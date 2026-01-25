import React, { useState, useEffect } from 'react';
import { base44 } from '@/api/base44Client';
import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query';
import { Loader2, Calendar, Filter, Download, Users } from 'lucide-react';
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from "@/components/ui/select";
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card";
import { Table, TableBody, TableCell, TableHead, TableHeader, TableRow } from "@/components/ui/table";
import { Badge } from "@/components/ui/badge";
import moment from 'moment';

import PageHeader from '@/components/common/PageHeader';
import AttendanceCard from '@/components/attendance/AttendanceCard';
import EmptyState from '@/components/common/EmptyState';
import ExportButton from '@/components/export/ExportButton';

export default function Attendance() {
  const [user, setUser] = useState(null);
  const [dateFilter, setDateFilter] = useState(moment().format('YYYY-MM-DD'));
  const [statusFilter, setStatusFilter] = useState('all');
  const [view, setView] = useState('cards');

  useEffect(() => {
    const loadUser = async () => {
      const currentUser = await base44.auth.me();
      setUser(currentUser);
    };
    loadUser();
  }, []);

  const isAdmin = user?.role === 'admin' || user?.user_role === 'owner' || user?.user_role === 'admin';

  const { data: attendance = [], isLoading } = useQuery({
    queryKey: ['attendance', dateFilter],
    queryFn: () => base44.entities.Attendance.filter({ date: dateFilter }),
  });

  // Filter attendance based on user role and filters
  const filteredAttendance = attendance.filter(record => {
    const statusMatch = statusFilter === 'all' || record.status === statusFilter;
    const userMatch = isAdmin || record.staff_email === user?.email;
    return statusMatch && userMatch;
  });

  const statusStyles = {
    punched_in: 'bg-emerald-100 text-emerald-700',
    punched_out: 'bg-blue-100 text-blue-700',
    absent: 'bg-red-100 text-red-700'
  };

  if (!user) {
    return (
      <div className="min-h-screen flex items-center justify-center bg-slate-50">
        <Loader2 className="w-8 h-8 animate-spin text-indigo-600" />
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-slate-50 p-4 sm:p-6 lg:p-8">
      <div className="max-w-7xl mx-auto">
        <PageHeader
          title="Attendance Records"
          subtitle={isAdmin ? "View and manage staff attendance" : "Your attendance history"}
        >
          {filteredAttendance.length > 0 && (
            <ExportButton 
              data={filteredAttendance} 
              filename="attendance_records"
              entityType="Attendance"
            />
          )}
        </PageHeader>

        {/* Filters */}
        <Card className="mb-6 border-0 shadow-sm">
          <CardContent className="p-4">
            <div className="flex flex-col sm:flex-row gap-4">
              <div className="flex items-center gap-2 flex-1">
                <Calendar className="w-5 h-5 text-slate-400" />
                <Input
                  type="date"
                  value={dateFilter}
                  onChange={(e) => setDateFilter(e.target.value)}
                  className="max-w-xs"
                />
              </div>
              
              <div className="flex items-center gap-2">
                <Filter className="w-5 h-5 text-slate-400" />
                <Select value={statusFilter} onValueChange={setStatusFilter}>
                  <SelectTrigger className="w-40">
                    <SelectValue />
                  </SelectTrigger>
                  <SelectContent>
                    <SelectItem value="all">All Status</SelectItem>
                    <SelectItem value="punched_in">Punched In</SelectItem>
                    <SelectItem value="punched_out">Punched Out</SelectItem>
                    <SelectItem value="absent">Absent</SelectItem>
                  </SelectContent>
                </Select>
              </div>

              <div className="flex gap-2">
                <Button
                  variant={view === 'cards' ? 'default' : 'outline'}
                  size="sm"
                  onClick={() => setView('cards')}
                  className={view === 'cards' ? 'bg-indigo-600' : ''}
                >
                  Cards
                </Button>
                <Button
                  variant={view === 'table' ? 'default' : 'outline'}
                  size="sm"
                  onClick={() => setView('table')}
                  className={view === 'table' ? 'bg-indigo-600' : ''}
                >
                  Table
                </Button>
              </div>
            </div>
          </CardContent>
        </Card>

        {/* Summary Stats */}
        {isAdmin && (
          <div className="grid grid-cols-3 gap-4 mb-6">
            <Card className="border-0 shadow-sm">
              <CardContent className="p-4 text-center">
                <p className="text-2xl font-bold text-emerald-600">
                  {filteredAttendance.filter(a => a.status === 'punched_in').length}
                </p>
                <p className="text-sm text-slate-500">Currently In</p>
              </CardContent>
            </Card>
            <Card className="border-0 shadow-sm">
              <CardContent className="p-4 text-center">
                <p className="text-2xl font-bold text-blue-600">
                  {filteredAttendance.filter(a => a.status === 'punched_out').length}
                </p>
                <p className="text-sm text-slate-500">Completed</p>
              </CardContent>
            </Card>
            <Card className="border-0 shadow-sm">
              <CardContent className="p-4 text-center">
                <p className="text-2xl font-bold text-slate-600">
                  {filteredAttendance.length}
                </p>
                <p className="text-sm text-slate-500">Total Records</p>
              </CardContent>
            </Card>
          </div>
        )}

        {/* Content */}
        {isLoading ? (
          <div className="flex items-center justify-center py-16">
            <Loader2 className="w-8 h-8 animate-spin text-indigo-600" />
          </div>
        ) : filteredAttendance.length === 0 ? (
          <EmptyState
            icon={Users}
            title="No attendance records"
            description={`No records found for ${moment(dateFilter).format('MMMM D, YYYY')}`}
          />
        ) : view === 'cards' ? (
          <div className="grid sm:grid-cols-2 lg:grid-cols-3 gap-4">
            {filteredAttendance.map(record => (
              <AttendanceCard key={record.id} attendance={record} />
            ))}
          </div>
        ) : (
          <Card className="border-0 shadow-sm overflow-hidden">
            <Table>
              <TableHeader>
                <TableRow className="bg-slate-50">
                  <TableHead>Staff</TableHead>
                  <TableHead>Date</TableHead>
                  <TableHead>Punch In</TableHead>
                  <TableHead>Punch Out</TableHead>
                  <TableHead>Status</TableHead>
                  <TableHead>Location</TableHead>
                </TableRow>
              </TableHeader>
              <TableBody>
                {filteredAttendance.map(record => (
                  <TableRow key={record.id}>
                    <TableCell>
                      <div>
                        <p className="font-medium">{record.staff_name}</p>
                        <p className="text-sm text-slate-500">{record.staff_email}</p>
                      </div>
                    </TableCell>
                    <TableCell>{moment(record.date).format('MMM D, YYYY')}</TableCell>
                    <TableCell>{record.punch_in_time || '—'}</TableCell>
                    <TableCell>{record.punch_out_time || '—'}</TableCell>
                    <TableCell>
                      <Badge className={statusStyles[record.status]}>
                        {record.status?.replace(/_/g, ' ')}
                      </Badge>
                    </TableCell>
                    <TableCell>
                      {record.punch_in_location ? (
                        <span className="text-xs text-slate-500">
                          {record.punch_in_location.latitude?.toFixed(4)}, {record.punch_in_location.longitude?.toFixed(4)}
                        </span>
                      ) : '—'}
                    </TableCell>
                  </TableRow>
                ))}
              </TableBody>
            </Table>
          </Card>
        )}
      </div>
    </div>
  );
}
